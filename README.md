@extends('layouts.profile')
@section('main')

<style>
  /* ── SIDEBAR ── */
  .sidebar {
    background: #1e2d5a;
    border-radius: 14px;
    overflow: hidden;
  }
  .sidebar-link {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 18px;
    font-size: 14px;
    font-weight: 600;
    color: rgba(255,255,255,0.65);
    transition: 0.2s;
    text-decoration: none;
    border-radius: 10px;
    margin: 2px 10px;
    cursor: pointer;
  }
  .sidebar-link:hover { background: rgba(255,255,255,0.08); color: #fff; }
  .sidebar-link.active { background: #2550d4; color: #fff; }
  .sidebar-link.logout:hover { color: #fca5a5; background: rgba(239,68,68,0.15); }
  @media (max-width: 768px) { .sidebar { border-radius: 5px; } }

  /* ── ORDERS ── */
  .order-card {
    background: #fff;
    border: 1px solid #e8eef7;
    border-radius: 14px;
    padding: 1.25rem 1.5rem;
    margin-bottom: 1rem;
    transition: box-shadow .18s;
  }
  .order-card:hover { box-shadow: 0 4px 20px rgba(59,130,246,.08); }
  .order-number { font-weight: 800; color: #1e293b; font-size: 1rem; }
  .order-meta   { color: #94a3b8; font-size: .8rem; margin-top: .15rem; }
  .order-total  { font-weight: 800; color: #1e293b; font-size: 1.05rem; }

  .order-thumb {
    width: 52px; height: 52px;
    border-radius: 10px;
    object-fit: cover;
    background: #e2e8f0;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem;
    border: 1px solid #e2e8f0;
    overflow: hidden;
  }
  .order-thumb-more {
    width: 52px; height: 52px;
    border-radius: 10px;
    background: #f1f5f9;
    border: 1px solid #e2e8f0;
    display: flex; align-items: center; justify-content: center;
    font-size: .82rem; font-weight: 700; color: #64748b;
  }

  .btn-view-details {
    border: 1px solid #d1d5db;
    background: #fff;
    color: #374151;
    border-radius: 8px;
    padding: .4rem 1rem;
    font-size: .82rem;
    font-weight: 600;
    cursor: pointer;
    transition: background .18s;
  }
  .btn-view-details:hover { background: #f9fafb; }
  .btn-leave-review {
    border: 1px solid #d1d5db;
    background: #fff;
    color: #374151;
    border-radius: 8px;
    padding: .4rem 1rem;
    font-size: .82rem;
    font-weight: 600;
    cursor: pointer;
    transition: background .18s;
  }
  .btn-leave-review:hover { background: #f9fafb; }

  /* Status badges */
  .badge-delivered  { background: #dcfce7; color: #16a34a; font-size: .75rem; font-weight: 700; padding: .3rem .75rem; border-radius: 20px; }
  .badge-shipped    { background: #faf5ff; color: #9333ea; font-size: .75rem; font-weight: 700; padding: .3rem .75rem; border-radius: 20px; }
  .badge-processing { background: #eff6ff; color: #3b82f6; font-size: .75rem; font-weight: 700; padding: .3rem .75rem; border-radius: 20px; }
  .badge-pending    { background: #fffbeb; color: #d97706; font-size: .75rem; font-weight: 700; padding: .3rem .75rem; border-radius: 20px; }
  .badge-cancelled  { background: #fef2f2; color: #dc2626; font-size: .75rem; font-weight: 700; padding: .3rem .75rem; border-radius: 20px; }

  /* ── WISHLIST ── */
  .wish-card {
    background: #fff;
    border: 1px solid #e8eef7;
    border-radius: 14px;
    padding: 1rem;
    display: flex;
    align-items: center;
    gap: 1rem;
    transition: box-shadow .18s;
  }
  .wish-card:hover { box-shadow: 0 4px 20px rgba(59,130,246,.08); }
  .wish-thumb {
    width: 72px; height: 72px;
    border-radius: 10px;
    object-fit: cover;
    background: #e2e8f0;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.8rem;
    flex-shrink: 0;
    overflow: hidden;
  }
  .wish-cat   { color: #3b82f6; font-size: .75rem; font-weight: 600; margin-bottom: .2rem; }
  .wish-name  { font-weight: 700; color: #1e293b; font-size: .92rem; margin-bottom: .25rem; }
  .wish-rating { color: #f59e0b; font-size: .78rem; font-weight: 600; }
  .wish-price { font-weight: 800; color: #1e293b; font-size: .95rem; }
  .btn-add-cart {
    background: #3b82f6;
    color: #fff;
    border: none;
    border-radius: 8px;
    padding: .45rem 1rem;
    font-size: .82rem;
    font-weight: 600;
    cursor: pointer;
    transition: background .18s;
    white-space: nowrap;
  }
  .btn-add-cart:hover { background: #2563eb; }
  .btn-wish-remove {
    background: none;
    border: none;
    color: #ef4444;
    font-size: 1.1rem;
    cursor: pointer;
    padding: .2rem;
    line-height: 1;
    transition: transform .18s;
  }
  .btn-wish-remove:hover { transform: scale(1.2); }

  /* ── SETTINGS ── */
  .settings-card {
    background: #fff;
    border: 1px solid #e8eef7;
    border-radius: 14px;
    padding: 1.5rem;
    margin-bottom: 1rem;
  }
  .settings-card-title {
    font-weight: 700;
    color: #1e293b;
    font-size: .95rem;
    display: flex;
    align-items: center;
    gap: .5rem;
  }
  .btn-edit-link {
    background: none;
    border: none;
    color: #64748b;
    font-size: .8rem;
    display: flex;
    align-items: center;
    gap: .3rem;
    cursor: pointer;
    padding: 0;
    transition: color .18s;
  }
  .btn-edit-link:hover { color: #3b82f6; }
  .info-tile {
    background: #f8faff;
    border: 1px solid #e8eef7;
    border-radius: 10px;
    padding: .85rem 1rem;
  }
  .info-tile .label {
    color: #94a3b8;
    font-size: .72rem;
    margin-bottom: .25rem;
  }
  .info-tile .value {
    color: #1e293b;
    font-size: .9rem;
    font-weight: 600;
  }
  .sec-btn {
    width: 100%;
    text-align: left;
    border-radius: 10px;
    padding: .9rem 1.1rem;
    font-size: .875rem;
    font-weight: 500;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #e8eef7;
    background: #f8faff;
    color: #374151;
    transition: background .18s;
    cursor: pointer;
    margin-bottom: .5rem;
  }
  .sec-btn:last-child { margin-bottom: 0; }
  .sec-btn:hover { background: #eef2ff; }
  .sec-btn.danger {
    background: #fff5f5;
    border-color: #fecdd3;
    color: #ef4444;
  }
  .sec-btn.danger:hover { background: #fee2e2; }

  /* ── Shared ── */
  .section-title {
    color: #1e293b;
    font-weight: 700;
    font-size: 1.25rem;
    margin-bottom: 1.25rem;
  }
  .empty-state { text-align: center; padding: 3rem 1rem; color: #94a3b8; }
  .empty-state i { font-size: 2.5rem; display: block; margin-bottom: .75rem; }
</style>

<div class="row g-4 align-items-start">

  {{-- ═══════════════════════════════
       SIDEBAR
  ═══════════════════════════════ --}}
  <aside class="sidebar col-12 col-md-4 col-lg-3 mb-4 w-100">

    {{-- Profile --}}
    <div class="text-center p-4 border-bottom border-light border-opacity-10">
      <div class="mx-auto mb-3 d-flex align-items-center justify-content-center"
           style="width:64px;height:64px;border-radius:50%;background:#4e85f4;
                  color:#fff;font-size:24px;font-weight:800;
                  box-shadow:0 0 0 4px rgba(78,133,244,0.28);">
        {{ strtoupper(substr($user->first_name, 0, 1)) }}
      </div>
      <p class="text-white fw-bold mb-0" style="font-size:.95rem;">
        {{ $user->first_name }} {{ $user->last_name }}
      </p>
      <p class="text-white-50 small mb-2">
        {{ $user->email }}
      </p>
      <span class="badge bg-light text-dark px-3 py-2" style="font-size:.75rem;">
        ⭐ Hobby Enthusiast
      </span>
    </div>

    {{-- Nav --}}
    <nav class="py-3" role="tablist">
      <a class="sidebar-link active"
         data-bs-toggle="tab"
         href="#orders"
         role="tab">
        <i class="fa-solid fa-box-open"></i>
        My Orders
      </a>
      <a class="sidebar-link"
         data-bs-toggle="tab"
         href="#wishlist"
         role="tab">
        <i class="fa-regular fa-heart"></i>
        Wishlist
      </a>
      <a class="sidebar-link"
         data-bs-toggle="tab"
         href="#settings"
         role="tab">
        <i class="fa-solid fa-gear"></i>
        Settings
      </a>
      <div class="mx-3 my-1" style="border-top:1px solid rgba(255,255,255,0.1);"></div>
      <form action="{{ route('logout') }}" method="POST">
        @csrf
        <button type="submit"
                class="sidebar-link logout w-100 border-0 bg-transparent text-start">
          <i class="fa-solid fa-right-from-bracket"></i>
          Logout
        </button>
      </form>
    </nav>

  </aside>

  {{-- ═══════════════════════════════
       TAB CONTENT
  ═══════════════════════════════ --}}
  <div class="col-12 col-md-8 col-lg-9">
    <div class="tab-content" id="accountTabContent">

      {{-- ================= ORDERS ================= --}}
      <div class="tab-pane fade show active" id="orders" role="tabpanel">

        <div class="section-title">My Orders</div>

        @if(isset($orders) && count($orders) > 0)
          @foreach($orders as $order)
            @php
              $badgeClass = match($order->status ?? '') {
                'Delivered'  => 'badge-delivered',
                'Shipped'    => 'badge-shipped',
                'Processing' => 'badge-processing',
                'Pending'    => 'badge-pending',
                'Cancelled'  => 'badge-cancelled',
                default      => 'badge-pending',
              };
            @endphp
            <div class="order-card">

              {{-- Top row: ID, status, total --}}
              <div class="d-flex justify-content-between align-items-start mb-2">
                <div>
                  <span class="order-number me-2">
                    ORD-{{ str_pad($order->id, 3, '0', STR_PAD_LEFT) }}
                  </span>
                  <span class="{{ $badgeClass }}">{{ $order->status ?? 'Pending' }}</span>
                  <div class="order-meta mt-1">
                    {{ \Carbon\Carbon::parse($order->created_at)->format('Y-m-d') }}
                    · {{ $order->items_count ?? count($order->items ?? []) }} item(s)
                  </div>
                </div>
                <div class="order-total">
                  ₱{{ number_format($order->total ?? $order->price, 2) }}
                </div>
              </div>

              {{-- Item thumbnails --}}
              @if(isset($order->items) && count($order->items) > 0)
                <div class="d-flex gap-2 mb-3">
                  @foreach($order->items->take(2) as $item)
                    <div class="order-thumb">
                      @if(isset($item->image))
                        <img src="{{ asset('storage/'.$item->image) }}"
                             alt="{{ $item->name }}"
                             style="width:100%;height:100%;object-fit:cover;"/>
                      @else
                        {{ $item->emoji ?? '📦' }}
                      @endif
                    </div>
                  @endforeach
                  @if(count($order->items) > 2)
                    <div class="order-thumb-more">
                      +{{ count($order->items) - 2 }}
                    </div>
                  @endif
                </div>
              @endif

              {{-- Action buttons --}}
              <div class="d-flex gap-2 flex-wrap">
                <button class="btn-view-details">View Details</button>
                @if(($order->status ?? '') === 'Delivered')
                  <button class="btn-leave-review">Leave Review</button>
                @endif
              </div>

            </div>
          @endforeach
        @else
          <div class="empty-state">
            <i class="fa-solid fa-inbox"></i>
            No orders yet. Start shopping!
          </div>
        @endif

      </div>

      {{-- ================= WISHLIST ================= --}}
      <div class="tab-pane fade" id="wishlist" role="tabpanel">

        <div class="section-title">My Wishlist</div>

        @if(isset($wishlist) && count($wishlist) > 0)
          <div class="row g-3">
            @foreach($wishlist as $item)
              <div class="col-12 col-lg-6">
                <div class="wish-card">

                  {{-- Thumbnail --}}
                  <div class="wish-thumb">
                    @if(isset($item->image))
                      <img src="{{ asset('storage/'.$item->image) }}"
                           alt="{{ $item->name }}"
                           style="width:100%;height:100%;object-fit:cover;"/>
                    @else
                      {{ $item->emoji ?? '🎁' }}
                    @endif
                  </div>

                  {{-- Info --}}
                  <div class="flex-grow-1 min-width-0">
                    <div class="wish-cat">{{ $item->cat ?? $item->category ?? '' }}</div>
                    <div class="wish-name">{{ $item->name }}</div>
                    <div class="wish-rating">
                      ⭐ {{ $item->rating ?? '—' }}
                    </div>
                  </div>

                  {{-- Price + actions --}}
                  <div class="d-flex flex-column align-items-end gap-2 flex-shrink-0">
                    <div class="wish-price">₱{{ number_format($item->price, 2) }}</div>
                    <div class="d-flex align-items-center gap-2">
                      <button class="btn-add-cart">Add to Cart</button>
                      <button class="btn-wish-remove" title="Remove from wishlist">
                        <i class="fa-solid fa-heart"></i>
                      </button>
                    </div>
                  </div>

                </div>
              </div>
            @endforeach
          </div>
        @else
          <div class="empty-state">
            <i class="fa-regular fa-heart"></i>
            Your wishlist is empty.
          </div>
        @endif

      </div>

      {{-- ================= SETTINGS ================= --}}
      <div class="tab-pane fade" id="settings" role="tabpanel">

        <div class="section-title">Account Settings</div>

        {{-- Personal Information --}}
        <div class="settings-card">
          <div class="d-flex align-items-center justify-content-between mb-3">
            <div class="settings-card-title">
              <i class="fa-regular fa-user text-secondary"></i>
              Personal Information
            </div>
            <button class="btn-edit-link">
              <i class="fa-solid fa-pen-to-square"></i> Edit
            </button>
          </div>
          <div class="row g-2">
            <div class="col-12 col-sm-6">
              <div class="info-tile">
                <div class="label">Full Name</div>
                <div class="value">{{ $user->first_name }} {{ $user->last_name }}</div>
              </div>
            </div>
            <div class="col-12 col-sm-6">
              <div class="info-tile">
                <div class="label">Email</div>
                <div class="value">{{ $user->email }}</div>
              </div>
            </div>
            @if(isset($user->phone))
              <div class="col-12 col-sm-6">
                <div class="info-tile">
                  <div class="label">Phone</div>
                  <div class="value">{{ $user->phone }}</div>
                </div>
              </div>
            @endif
            @if(isset($user->birthday))
              <div class="col-12 col-sm-6">
                <div class="info-tile">
                  <div class="label">Birthday</div>
                  <div class="value">
                    {{ \Carbon\Carbon::parse($user->birthday)->format('M d, Y') }}
                  </div>
                </div>
              </div>
            @endif
          </div>
        </div>

        {{-- Security --}}
        <div class="settings-card">
          <div class="settings-card-title mb-3">
            🔒 Security
          </div>
          <button class="sec-btn">
            Change Password
            <i class="fa-solid fa-chevron-right" style="font-size:.75rem;color:#94a3b8;"></i>
          </button>
          <button class="sec-btn danger">
            Delete Account
            <i class="fa-solid fa-chevron-right" style="font-size:.75rem;"></i>
          </button>
        </div>

      </div>{{-- end settings --}}

    </div>{{-- end tab-content --}}
  </div>

</div>{{-- end row --}}

@endsection
